# ClaudeDebug スナップショット

## 🟡 現状: YELLOW

**生成**: 2026-04-27T10:40:01.458600+09:00

### 次に取るべきアクション
> YELLOW監視: FINAL_MISSING×60 (24h)

### 検出された問題
- 🟡 FINAL_MISSING×60 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_BET_VOLUME_DROP  ×39  [2026-04-27T10:00:24]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×1  [2026-04-27T09:35:06]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ ROI_STAT  ×1  [2026-04-27T06:00:08]
- key: `ROI_STAT|S00: n=54 hit%=25.9% hit_CI[Bonf]=[12.8,45.5]% ROI=0.92 ROI_boot95=[0.44,1.43]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-04-27T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=54<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-04-27T06:00:08]
- key: `ORPHAN_SCAN|45 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-27T06:00:08]
- key: `CALIBRATION_LIVE|bt=win: n=54 pred=0.4397 actual=0.2593 error=+0.1805 (+41%) brier=0.2339 [OVERCO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-27T06:00:08]
- key: `CALIBRATION_LIVE|S00(win): n=54 pred=0.4397 hit=0.2593 cal_err=+0.1805 brier=0.2339 BSS=-0.22 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-27T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=21 pred=0.4462 actual=0.2857 gap=+0.1605`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-27T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.50+: n=24 pred=0.5328 actual=0.2917 gap=+0.2412`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-27T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-27T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-27T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=906 bet=300 odds=14.2 payout=360 ratio=0.08`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-27T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=913 bet=300 odds=4.6 payout=2550 ratio=1.85`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-27T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=917 bet=300 odds=6.2 payout=390 ratio=0.21`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×52  [2026-04-26T11:34:40]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.27MB / last modified 2026-04-27T10:39:45.751564+09:00

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
 24/30 parsed
2026-04-27 10:38:46,735 [INFO] scraper: odds2f: 13/15 parsed
2026-04-27 10:38:47,855 [INFO] scraper: odds_win: 2/6 parsed
2026-04-27 10:38:47,855 [INFO] scraper: fetch_race 08/2: boats=6 odds=176/191
2026-04-27 10:38:47,863 [INFO] predictor: CALIBRATION_MODE=on
2026-04-27 10:38:47,863 [INFO] predictor: combos: {'win': 2, '2t': 24, '3t': 120}
2026-04-27 10:38:47,871 [INFO] run_cycle: fetched 08/2 [scan]: 146 combos
2026-04-27 10:38:47,974 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-27 10:39:05,462 [INFO] run_cycle: === run_cycle 10:39:05 ===
2026-04-27 10:39:05,462 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-27 10:39:05,462 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-27 10:39:05,508 [INFO] predictor: Models loaded OK
2026-04-27 10:39:16,579 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=1&jcd=13&hd=20260427: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-04-27 10:39:27,633 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=1&jcd=13&hd=20260427: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-04-27 10:39:42,055 [INFO] scraper: odds3t: 120/120 parsed
2026-04-27 10:39:43,139 [INFO] scraper: odds3f: 20/20 parsed
2026-04-27 10:39:44,245 [INFO] scraper: odds2t: 30/30 parsed
2026-04-27 10:39:44,246 [INFO] scraper: odds2f: 14/15 parsed
2026-04-27 10:39:45,341 [INFO] scraper: odds_win: 3/6 parsed
2026-04-27 10:39:45,342 [INFO] scraper: fetch_race 13/1: boats=6 odds=187/191
2026-04-27 10:39:45,354 [INFO] predictor: CALIBRATION_MODE=on
2026-04-27 10:39:45,354 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-04-27 10:39:45,361 [INFO] run_cycle: fetched 13/1 [final]: 153 combos
2026-04-27 10:39:45,643 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 31
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 31
  }
]
```

## Phase別通知記録 (24h)
{'final': 11, 'result': 7, 'scan': 13}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 149
  FINAL_MISSING: 60
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 52 | 14 | 15,600 | 14,940 | -660 | 0.958 |

## 直近アラート (24h・新しい順)
```
[10:00:24] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 1.6, "baseline_n_days": 5, "baseline_stdev": 0.5, "hour": 10, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -2.92}
[09:35:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 628}
[23:57:05] FINAL_MISSING: {"deadline": "2026-04-26T13:20:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042616061320", "sid": "S00"}
[23:32:05] FINAL_MISSING: {"deadline": "2026-04-26T14:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042604091456", "sid": "S00"}
[23:24:06] FINAL_MISSING: {"deadline": "2026-04-26T11:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042608041147", "sid": "S00"}
[23:21:05] FINAL_MISSING: {"deadline": "2026-04-26T16:46:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042612041646", "sid": "S00"}
[23:21:05] FINAL_MISSING: {"deadline": "2026-04-26T15:46:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042607021546", "sid": "S00"}
[23:12:05] FINAL_MISSING: {"deadline": "2026-04-26T10:36:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042613011036", "sid": "S00"}
[22:56:05] FINAL_MISSING: {"deadline": "2026-04-26T13:20:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042616061320", "sid": "S00"}
[22:31:22] FINAL_MISSING: {"deadline": "2026-04-26T14:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042604091456", "sid": "S00"}
```

## 本日残レース: 175件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 17件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 047R | win | 1 | 0.5334 | 5.5 | 2.93 | 300 | scan=- drift=- | 13:50:30 |
| S00 | 046R | win | 1 | 0.2290 | 23.2 | 5.31 | 300 | scan=22.5 drift=+3.1% | 13:19:43 |
| S00 | 219R | win | 1 | 0.5735 | 4.9 | 2.81 | 300 | scan=9.7 drift=-49.5% | 12:35:32 |
| S00 | 044R | win | 1 | 0.4989 | 5.1 | 2.54 | 300 | scan=5.0 drift=+2.0% | 12:19:20 |
| S00 | 164R | win | 1 | 0.5123 | 6.2 | 3.18 | 300 | scan=- drift=- | 12:17:21 |
| S00 | 041R | win | 1 | 0.5174 | 5.1 | 2.64 | 300 | scan=6.0 drift=-15.0% | 10:52:45 |
| S00 | 082R | win | 1 | 0.5174 | 4.6 | 2.38 | 300 | scan=- drift=- | 10:44:20 |
| S00 | 206R | win | 1 | 0.5990 | 5.7 | 3.41 | 300 | scan=- drift=- | 17:29:20 |
| S00 | 153R | win | 1 | 0.4111 | 4.6 | 1.89 | 300 | scan=6.0 drift=-23.3% | 16:21:44 |
| S00 | 152R | win | 1 | 0.5123 | 17.2 | 8.81 | 300 | scan=6.7 drift=+156.7% | 15:49:29 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 29 | +11.9% | -68.2% | +156.7% | 12 | 6 | 24 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 495.1s |
| **Latency** (scan→final max) | 609.2s |
| **Traffic** (notifications 24h) | 31 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 54 | 0.4397 | 0.2593 | +0.1805 | 🟡+41% | 0.2339 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 54 | 0.4397 | 0.2593 | 0.2339 | 🔴-0.22 | 0.922 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 23 | 0.4367 | 0.2609 | 🔴+0.1758 |
| 0.50+ | 24 | 0.5328 | 0.2917 | 🔴+0.2412 |

## Settlement Ratio データ品質

- 学習済み: 0バンド / fallback: 16バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 4 | 0.35 |
| win | <10.0 | ⚠️fallback | 8 | 0.32 |
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
_auto-generated by claude_snapshot.py at 2026-04-27T10:40:01.458600+09:00_