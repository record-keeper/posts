# ClaudeDebug スナップショット

## 🟡 現状: YELLOW

**生成**: 2026-04-24T13:10:01.426638+09:00

### 次に取るべきアクション
> YELLOW監視: FINAL_MISSING×51 (24h)

### 検出された問題
- 🟡 FINAL_MISSING×51 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×20  [2026-04-24T12:12:35]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×4  [2026-04-24T11:17:36]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×21  [2026-04-24T11:00:36]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-04-24T06:00:06]
- key: `ORPHAN_SCAN|19 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-24T06:00:06]
- key: `CALIBRATION_LIVE|bt=win: n=25 pred=0.4263 actual=0.2000 error=+0.2263 (+53%) brier=0.2112 [OVERCO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-24T06:00:06]
- key: `CALIBRATION_LIVE|S00(win): n=25 pred=0.4263 hit=0.2000 cal_err=+0.2263 brier=0.2112 BSS=-0.32 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-24T06:00:06]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=10 pred=0.4423 actual=0.3000 gap=+0.1423`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-24T06:00:06]
- key: `CALIBRATION_LIVE|decile 0.50+: n=10 pred=0.5301 actual=0.2000 gap=+0.3301`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-24T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-24T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.09MB / last modified 2026-04-24T13:09:57.795313+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
d=20260424: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-04-24 13:09:40,051 [INFO] scraper: odds3t: 120/120 parsed
2026-04-24 13:09:41,145 [INFO] scraper: odds3f: 20/20 parsed
2026-04-24 13:09:42,230 [INFO] scraper: odds2t: 30/30 parsed
2026-04-24 13:09:42,231 [INFO] scraper: odds2f: 15/15 parsed
2026-04-24 13:09:43,343 [INFO] scraper: odds_win: 6/6 parsed
2026-04-24 13:09:43,343 [INFO] scraper: fetch_race 14/10: boats=6 odds=191/191
2026-04-24 13:09:43,355 [INFO] predictor: CALIBRATION_MODE=on
2026-04-24 13:09:43,355 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-04-24 13:09:43,362 [INFO] run_cycle: fetched 14/10 [final]: 156 combos
2026-04-24 13:09:46,941 [INFO] scraper: odds3t: 120/120 parsed
2026-04-24 13:09:48,049 [INFO] scraper: odds3f: 20/20 parsed
2026-04-24 13:09:49,157 [INFO] scraper: odds2t: 30/30 parsed
2026-04-24 13:09:49,158 [INFO] scraper: odds2f: 15/15 parsed
2026-04-24 13:09:50,297 [INFO] scraper: odds_win: 6/6 parsed
2026-04-24 13:09:50,297 [INFO] scraper: fetch_race 17/6: boats=6 odds=191/191
2026-04-24 13:09:50,306 [INFO] predictor: CALIBRATION_MODE=on
2026-04-24 13:09:50,308 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-04-24 13:09:50,316 [INFO] run_cycle: fetched 17/6 [scan]: 156 combos
2026-04-24 13:09:54,024 [INFO] scraper: odds3t: 120/120 parsed
2026-04-24 13:09:55,274 [INFO] scraper: odds3f: 20/20 parsed
2026-04-24 13:09:56,534 [INFO] scraper: odds2t: 30/30 parsed
2026-04-24 13:09:56,535 [INFO] scraper: odds2f: 15/15 parsed
2026-04-24 13:09:57,666 [INFO] scraper: odds_win: 3/6 parsed
2026-04-24 13:09:57,666 [INFO] scraper: fetch_race 04/6: boats=6 odds=188/191
2026-04-24 13:09:57,675 [INFO] predictor: CALIBRATION_MODE=on
2026-04-24 13:09:57,675 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-04-24 13:09:57,683 [INFO] run_cycle: fetched 04/6 [scan]: 153 combos
2026-04-24 13:09:57,776 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 38
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 38
  }
]
```

## Phase別通知記録 (24h)
{'final': 12, 'result': 7, 'scan': 19}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 201
  FINAL_MISSING: 51
  ANOMALY_SCAN_FINAL_RATIO: 9
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 29 | 6 | 8,700 | 7,020 | -1,680 | 0.807 |

## 直近アラート (24h・新しい順)
```
[12:57:30] FINAL_MISSING: {"deadline": "2026-04-24T11:27:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042409031127", "sid": "S00"}
[12:52:35] FINAL_MISSING: {"deadline": "2026-04-24T12:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042404041222", "sid": "S00"}
[12:38:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1084}
[12:37:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1085}
[12:36:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1075}
[12:34:43] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1047}
[12:33:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1046}
[12:32:29] FINAL_MISSING: {"deadline": "2026-04-24T11:02:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042414061102", "sid": "S00"}
[12:32:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1026}
[12:30:41] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1027}
```

## 本日残レース: 97件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 59件 締切済
- 通知発射: scan=10 nid / final=7 nid / result=4 nid
- predictions: 5 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 087R | win | 1 | 0.5476 | 9.7 | 5.31 | 300 | scan=4.5 drift=+115.6% | 13:07:32 |
| S00 | 164R | win | 1 | 0.4111 | 10.8 | 4.44 | 300 | scan=4.5 drift=+140.0% | 12:16:19 |
| S00 | 043R | win | 1 | 0.5476 | 28.5 | 15.61 | 300 | scan=- drift=- | 11:50:34 |
| S00 | 163R | win | 1 | 0.1371 | 5.1 | 0.70 | 300 | scan=6.7 drift=-23.9% | 11:47:22 |
| S00 | 042R | win | 1 | 0.4111 | 15.4 | 6.33 | 300 | scan=6.0 drift=+156.7% | 11:22:21 |
| S00 | 206R | win | 1 | 0.5735 | 4.7 | 2.70 | 300 | scan=6.7 drift=-29.9% | 17:41:21 |
| S00 | 1611R | win | 1 | 0.4111 | 4.0 | 1.64 | 300 | scan=8.7 drift=-54.0% | 16:07:32 |
| S00 | 226R | win | 1 | 0.4989 | 8.2 | 4.09 | 300 | scan=22.6 drift=-63.7% | 14:52:44 |
| S00 | 014R | win | 1 | 0.0156 | 45.3 | 0.71 | 300 | scan=- drift=- | 16:36:27 |
| S00 | 227R | win | 1 | 0.4111 | 4.6 | 1.89 | 300 | scan=- drift=- | 15:19:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 16 | +18.5% | -68.2% | +156.7% | 6 | 3 | 15 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 543.1s |
| **Latency** (scan→final max) | 616.2s |
| **Traffic** (notifications 24h) | 38 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 29 | 0.4195 | 0.2069 | +0.2126 | 🔴+51% | 0.2297 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 29 | 0.4195 | 0.2069 | 0.2297 | 🔴-0.40 | 0.807 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 14 | 0.4228 | 0.2143 | 🔴+0.2085 |
| 0.50+ | 11 | 0.5317 | 0.1818 | 🔴+0.3499 |

## Settlement Ratio データ品質

- 学習済み: 0バンド / fallback: 16バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 1 | 0.35 |
| win | <10.0 | ⚠️fallback | 4 | 0.32 |
| win | <20.0 | ⚠️fallback | 1 | 0.22 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-04-24T13:10:01.426638+09:00_