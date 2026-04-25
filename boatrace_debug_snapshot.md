# ClaudeDebug スナップショット

## 🟡 現状: YELLOW

**生成**: 2026-04-25T14:30:01.925358+09:00

### 次に取るべきアクション
> YELLOW監視: FINAL_MISSING×94 (24h)

### 検出された問題
- 🟡 FINAL_MISSING×94 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×56  [2026-04-25T13:33:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×14  [2026-04-25T12:45:48]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×39  [2026-04-25T11:40:35]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×15  [2026-04-25T10:00:25]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ ROI_STAT  ×1  [2026-04-25T06:00:07]
- key: `ROI_STAT|S00: n=36 hit%=25.0% hit_CI[Bonf]=[10.3,49.1]% ROI=0.94 ROI_boot95=[0.41,1.56]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-04-25T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=36<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-04-25T06:00:07]
- key: `ORPHAN_SCAN|28 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-25T06:00:07]
- key: `CALIBRATION_LIVE|bt=win: n=36 pred=0.4350 actual=0.2500 error=+0.1850 (+43%) brier=0.2324 [OVERCO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-25T06:00:07]
- key: `CALIBRATION_LIVE|S00(win): n=36 pred=0.4350 hit=0.2500 cal_err=+0.1850 brier=0.2324 BSS=-0.24 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-25T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=14 pred=0.4396 actual=0.2143 gap=+0.2254`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-25T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.50+: n=16 pred=0.5271 actual=0.3125 gap=+0.2146`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-25T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-25T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.21MB / last modified 2026-04-25T14:30:02.600582+09:00

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
sed
2026-04-25 14:28:31,591 [INFO] scraper: fetch_race 09/9: boats=6 odds=190/191
2026-04-25 14:28:31,594 [INFO] predictor: CALIBRATION_MODE=on
2026-04-25 14:28:31,594 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-04-25 14:28:31,598 [INFO] run_cycle: fetched 09/9 [final]: 155 combos
2026-04-25 14:28:35,148 [INFO] scraper: odds3t: 120/120 parsed
2026-04-25 14:28:36,235 [INFO] scraper: odds3f: 20/20 parsed
2026-04-25 14:28:37,333 [INFO] scraper: odds2t: 28/30 parsed
2026-04-25 14:28:37,334 [INFO] scraper: odds2f: 14/15 parsed
2026-04-25 14:28:38,420 [INFO] scraper: odds_win: 6/6 parsed
2026-04-25 14:28:38,420 [INFO] scraper: fetch_race 06/7: boats=6 odds=188/191
2026-04-25 14:28:38,422 [INFO] predictor: CALIBRATION_MODE=on
2026-04-25 14:28:38,422 [INFO] predictor: combos: {'win': 6, '2t': 28, '3t': 120}
2026-04-25 14:28:38,426 [INFO] run_cycle: fetched 06/7 [scan]: 154 combos
2026-04-25 14:28:38,574 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-25 14:29:05,609 [INFO] run_cycle: === run_cycle 14:29:05 ===
2026-04-25 14:29:05,609 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-25 14:29:05,609 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-25 14:29:05,654 [INFO] predictor: Models loaded OK
2026-04-25 14:29:18,189 [INFO] scraper: odds3t: 120/120 parsed
2026-04-25 14:29:19,277 [INFO] scraper: odds3f: 20/20 parsed
2026-04-25 14:29:20,419 [INFO] scraper: odds2t: 30/30 parsed
2026-04-25 14:29:20,420 [INFO] scraper: odds2f: 15/15 parsed
2026-04-25 14:29:21,490 [INFO] scraper: odds_win: 5/6 parsed
2026-04-25 14:29:21,490 [INFO] scraper: fetch_race 09/9: boats=6 odds=190/191
2026-04-25 14:29:21,502 [INFO] predictor: CALIBRATION_MODE=on
2026-04-25 14:29:21,502 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-04-25 14:29:21,509 [INFO] run_cycle: fetched 09/9 [final]: 155 combos
2026-04-25 14:29:21,758 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 42
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 42
  }
]
```

## Phase別通知記録 (24h)
{'final': 14, 'result': 12, 'scan': 16}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 206
  FINAL_MISSING: 94
  ANOMALY_BET_VOLUME_SPIKE: 3
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 11 | 12,600 | 11,280 | -1,320 | 0.895 |

## 直近アラート (24h・新しい順)
```
[14:29:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1247}
[14:28:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1238}
[14:27:26] FINAL_MISSING: {"deadline": "2026-04-25T13:57:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042522041357", "sid": "S00"}
[14:27:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1269}
[14:25:19] FINAL_MISSING: {"deadline": "2026-04-25T11:53:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042504031153", "sid": "S00"}
[14:24:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1263}
[14:22:46] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1245}
[14:21:34] FINAL_MISSING: {"deadline": "2026-04-25T11:49:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042516031149", "sid": "S00"}
[14:21:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1226}
[14:17:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1204}
```

## 本日残レース: 96件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 96件 締切済
- 通知発射: scan=13 nid / final=11 nid / result=8 nid
- predictions: 8 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 223R | win | 1 | 0.5891 | 4.3 | 2.53 | 300 | scan=- drift=- | 13:28:21 |
| S00 | 086R | win | 1 | 0.4989 | 8.4 | 4.19 | 300 | scan=4.7 drift=+78.7% | 12:45:33 |
| S00 | 239R | win | 1 | 0.4111 | 4.0 | 1.64 | 300 | scan=- drift=- | 12:20:43 |
| S00 | 044R | win | 1 | 0.0920 | 10.2 | 0.94 | 300 | scan=20.0 drift=-49.0% | 12:20:35 |
| S00 | 164R | win | 1 | 0.1957 | 7.2 | 1.41 | 300 | scan=- drift=- | 12:16:22 |
| S00 | 093R | win | 1 | 0.4989 | 14.2 | 7.08 | 300 | scan=- drift=- | 11:23:20 |
| S00 | 041R | win | 1 | 0.4854 | 6.7 | 3.25 | 300 | scan=8.0 drift=-16.2% | 10:52:21 |
| S00 | 235R | win | 1 | 0.4111 | 9.5 | 3.91 | 300 | scan=9.5 drift=+0.0% | 10:15:21 |
| S00 | 078R | win | 1 | 0.5123 | 7.1 | 3.64 | 300 | scan=17.8 drift=-60.1% | 18:36:21 |
| S00 | 1610R | win | 1 | 0.5123 | 5.1 | 2.61 | 300 | scan=- drift=- | 15:34:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 23 | +11.8% | -68.2% | +156.7% | 9 | 5 | 20 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 412.6s |
| **Latency** (scan→final max) | 661.1s |
| **Traffic** (notifications 24h) | 42 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 44 | 0.4282 | 0.2500 | +0.1782 | 🟡+42% | 0.2275 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 44 | 0.4282 | 0.2500 | 0.2275 | 🔴-0.21 | 0.855 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 21 | 0.4350 | 0.2381 | 🔴+0.1969 |
| 0.50+ | 17 | 0.5307 | 0.2941 | 🔴+0.2366 |

## Settlement Ratio データ品質

- 学習済み: 0バンド / fallback: 16バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 2 | 0.35 |
| win | <10.0 | ⚠️fallback | 7 | 0.32 |
| win | <20.0 | ⚠️fallback | 2 | 0.22 |
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
_auto-generated by claude_snapshot.py at 2026-04-25T14:30:01.925358+09:00_