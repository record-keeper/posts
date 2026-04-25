# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-04-25T13:10:02.151382+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×2 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×93 (24h)
- 🔴 CALIBRATION_DRIFT×2 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×14  [2026-04-25T12:45:48]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×35  [2026-04-25T12:19:56]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

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

### 🔴 CALIBRATION_DRIFT  ×33  [2026-04-24T13:57:29]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.19MB / last modified 2026-04-25T13:09:36.158909+09:00

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
d
2026-04-25 13:09:20,055 [INFO] scraper: odds2f: 15/15 parsed
2026-04-25 13:09:21,162 [INFO] scraper: odds_win: 3/6 parsed
2026-04-25 13:09:21,162 [INFO] scraper: fetch_race 21/10: boats=6 odds=188/191
2026-04-25 13:09:21,174 [INFO] predictor: CALIBRATION_MODE=on
2026-04-25 13:09:21,174 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-04-25 13:09:21,181 [INFO] run_cycle: fetched 21/10 [final]: 153 combos
2026-04-25 13:09:24,761 [INFO] scraper: odds3t: 120/120 parsed
2026-04-25 13:09:25,881 [INFO] scraper: odds3f: 20/20 parsed
2026-04-25 13:09:27,078 [INFO] scraper: odds2t: 30/30 parsed
2026-04-25 13:09:27,079 [INFO] scraper: odds2f: 14/15 parsed
2026-04-25 13:09:28,208 [INFO] scraper: odds_win: 1/6 parsed
2026-04-25 13:09:28,208 [INFO] scraper: fetch_race 08/7: boats=6 odds=185/191
2026-04-25 13:09:28,218 [INFO] predictor: CALIBRATION_MODE=on
2026-04-25 13:09:28,218 [INFO] predictor: combos: {'win': 1, '2t': 30, '3t': 120}
2026-04-25 13:09:28,226 [INFO] run_cycle: fetched 08/7 [scan]: 151 combos
2026-04-25 13:09:31,687 [INFO] scraper: odds3t: 120/120 parsed
2026-04-25 13:09:32,791 [INFO] scraper: odds3f: 20/20 parsed
2026-04-25 13:09:33,896 [INFO] scraper: odds2t: 30/30 parsed
2026-04-25 13:09:33,897 [INFO] scraper: odds2f: 15/15 parsed
2026-04-25 13:09:34,991 [INFO] scraper: odds_win: 5/6 parsed
2026-04-25 13:09:34,991 [INFO] scraper: fetch_race 04/6: boats=6 odds=190/191
2026-04-25 13:09:35,001 [INFO] predictor: CALIBRATION_MODE=on
2026-04-25 13:09:35,001 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-04-25 13:09:35,009 [INFO] run_cycle: fetched 04/6 [scan]: 155 combos
2026-04-25 13:09:35,075 [INFO] race_id: notif: nid=2026042504061322 sid=S00 phase=scan rank=S
2026-04-25 13:09:35,482 [INFO] notifier: Discord notify OK (status=204)
2026-04-25 13:09:36,005 [INFO] notifier: Discord notify OK (status=204)
2026-04-25 13:09:36,053 [INFO] run_cycle: SCAN S00 平和島6R S
2026-04-25 13:09:36,141 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 47
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 47
  }
]
```

## Phase別通知記録 (24h)
{'final': 15, 'result': 13, 'scan': 19}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 162
  FINAL_MISSING: 93
  ANOMALY_SCAN_FINAL_RATIO: 5
  ANOMALY_BET_VOLUME_SPIKE: 4
  CALIBRATION_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 11 | 12,300 | 11,280 | -1,020 | 0.917 |

## 直近アラート (24h・新しい順)
```
[13:01:35] FINAL_MISSING: {"deadline": "2026-04-25T10:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042509011029", "sid": "S00"}
[12:58:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1207}
[12:56:07] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1198}
[12:48:35] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1213}
[12:47:21] FINAL_MISSING: {"deadline": "2026-04-25T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042508031116", "sid": "S00"}
[12:47:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1187}
[12:45:48] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1188}
[12:45:48] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 2.7, "baseline_n_days": 6, "baseline_stdev": 2.0, "hour": 12, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 7, "z_score": 2.2}
[12:44:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1193}
[12:43:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1215}
```

## 本日残レース: 124件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 68件 締切済
- 通知発射: scan=10 nid / final=8 nid / result=6 nid
- predictions: 7 / うち結果DB記録済: 6
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 086R | win | 1 | 0.4989 | 8.4 | 4.19 | 300 | scan=4.7 drift=+78.7% | 12:45:33 |
| S00 | 239R | win | 1 | 0.4111 | 4.0 | 1.64 | 300 | scan=- drift=- | 12:20:43 |
| S00 | 044R | win | 1 | 0.0920 | 10.2 | 0.94 | 300 | scan=20.0 drift=-49.0% | 12:20:35 |
| S00 | 164R | win | 1 | 0.1957 | 7.2 | 1.41 | 300 | scan=- drift=- | 12:16:22 |
| S00 | 093R | win | 1 | 0.4989 | 14.2 | 7.08 | 300 | scan=- drift=- | 11:23:20 |
| S00 | 041R | win | 1 | 0.4854 | 6.7 | 3.25 | 300 | scan=8.0 drift=-16.2% | 10:52:21 |
| S00 | 235R | win | 1 | 0.4111 | 9.5 | 3.91 | 300 | scan=9.5 drift=+0.0% | 10:15:21 |
| S00 | 078R | win | 1 | 0.5123 | 7.1 | 3.64 | 300 | scan=17.8 drift=-60.1% | 18:36:21 |
| S00 | 1610R | win | 1 | 0.5123 | 5.1 | 2.61 | 300 | scan=- drift=- | 15:34:32 |
| S00 | 168R | win | 1 | 0.5016 | 5.6 | 2.81 | 300 | scan=4.7 drift=+19.1% | 14:38:31 |

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
| **Latency** (scan→final avg) | 481.4s |
| **Latency** (scan→final max) | 661.1s |
| **Traffic** (notifications 24h) | 47 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 42 | 0.4227 | 0.2619 | +0.1608 | 🟡+38% | 0.2242 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 42 | 0.4227 | 0.2619 | 0.2242 | 🔴-0.16 | 0.895 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 20 | 0.4318 | 0.2500 | 🔴+0.1818 |
| 0.50+ | 16 | 0.5271 | 0.3125 | 🔴+0.2146 |

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
_auto-generated by claude_snapshot.py at 2026-04-25T13:10:02.151382+09:00_