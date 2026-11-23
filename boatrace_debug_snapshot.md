# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-23T09:00:02.345303+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×31 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×114 (24h)
- 🔴 PSI_DRIFT_DETECTED×31 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×2  [2026-11-23T08:55:53]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×41  [2026-11-23T08:04:07]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×41  [2026-11-23T08:04:07]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-23T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=25 hit%=20.0% ROI=0.82 (コスト 5,500/回収 4,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-11-23T06:00:11]
- key: `ROI_STAT|S00: n=81 hit%=24.7% hit_CI[Bonf]=[13.7,40.4]% ROI=0.61 ROI_boot95=[0.37,0.90]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-23T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-23T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=90 hit%=32.2% hit_CI[Bonf]=[20.0,47.4]% ROI=0.83 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-23T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=90<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-23T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=39 hit%=41.0% hit_CI[Bonf]=[21.9,63.3]% ROI=1.18 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-23T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=39<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-23T06:00:11]
- key: `ORPHAN_SCAN|253 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-23T06:00:11]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=40 hit%=45.0% ROI=1.12 (コスト 9,200/回収 10,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-23T06:00:11]
- key: `CALIBRATION_LIVE|bt=win: n=210 pred=0.4772 actual=0.3095 error=+0.1677 (+35%) brier=0.2343 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-23T06:00:11]
- key: `CALIBRATION_LIVE|S00(win): n=81 pred=0.4352 hit=0.2469 cal_err=+0.1883 brier=0.2137 BSS=-0.15 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-23T06:00:11]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=90 pred=0.4831 hit=0.3222 cal_err=+0.1609 brier=0.2379 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-23T06:00:11]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=39 pred=0.5506 hit=0.4103 cal_err=+0.1404 brier=0.2688 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-23T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=22 pred=0.3196 actual=0.1818 gap=+0.1378`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-23T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=58 pred=0.4470 actual=0.3448 gap=+0.1022`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-23T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.50+: n=120 pred=0.5466 actual=0.3417 gap=+0.2049`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-11-23T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=3323 bet=300 odds=7.1 payout=630 ratio=0.30`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.48MB / last modified 2026-11-23T08:59:33.385291+09:00

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
d OK
2026-11-23 08:58:33,759 [INFO] scraper: odds3t: 120/120 parsed
2026-11-23 08:58:43,869 [INFO] scraper: odds3f: 20/20 parsed
2026-11-23 08:58:54,882 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=2&jcd=14&hd=20261123: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-23 08:59:06,008 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=2&jcd=14&hd=20261123: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-23 08:59:19,055 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=2&jcd=14&hd=20261123: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-11-23 08:59:19,055 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=2&jcd=14&hd=20261123
2026-11-23 08:59:29,256 [INFO] scraper: odds_win: 5/6 parsed
2026-11-23 08:59:29,256 [INFO] scraper: fetch_race 14/2: boats=6 odds=145/191
2026-11-23 08:59:29,259 [INFO] predictor: CALIBRATION_MODE=on
2026-11-23 08:59:29,259 [INFO] predictor: combos: {'win': 5, '3t': 120}
2026-11-23 08:59:29,263 [INFO] run_cycle: fetched 14/2 [final]: 125 combos
2026-11-23 08:59:29,478 [INFO] race_id: notif: nid=2026112314020901 sid=S00 phase=final rank=A
2026-11-23 08:59:29,892 [INFO] notifier: Discord notify OK (status=204)
2026-11-23 08:59:31,097 [INFO] notifier: Discord notify OK (status=204)
2026-11-23 08:59:31,226 [INFO] run_cycle: FINAL S00 鳴門2R A
2026-11-23 08:59:32,285 [INFO] race_id: notif: nid=2026112314020901 sid=S01_NAKAANA1 phase=final rank=A
2026-11-23 08:59:32,716 [INFO] notifier: Discord notify OK (status=204)
2026-11-23 08:59:33,376 [INFO] notifier: Discord notify OK (status=204)
2026-11-23 08:59:33,429 [INFO] run_cycle: FINAL S01_NAKAANA1 鳴門2R A
2026-11-23 09:00:03,957 [INFO] scraper: odds3t: 120/120 parsed

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

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
{'final': 10, 'result': 5, 'scan': 16}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 238
  FINAL_MISSING: 114
  PSI_DRIFT_DETECTED: 31
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 9 | 3 | 2,700 | 1,860 | -840 | 0.689 |
| S01_NAKAANA1 | 17 | 6 | 3,400 | 2,920 | -480 | 0.859 |
| S02_TETSUBAN | 6 | 3 | 1,200 | 2,200 | +1,000 | 1.833 |

## 直近アラート (24h・新しい順)
```
[08:57:02] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 365}
[08:55:50] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 352}
[08:04:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:04:07] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 180, "n_recent": 30, "psi": 0.559}
[06:00:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:04] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 180, "n_recent": 30, "psi": 0.559}
[23:58:04] FINAL_MISSING: {"deadline": "2026-11-22T14:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112205091416", "sid": "S00"}
[23:53:04] FINAL_MISSING: {"deadline": "2026-11-22T12:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112210081209", "sid": "S00"}
[23:53:04] FINAL_MISSING: {"deadline": "2026-11-22T11:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112205021101", "sid": "S00"}
[23:42:04] FINAL_MISSING: {"deadline": "2026-11-22T13:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112202061300", "sid": "S00"}
```

## 本日残レース: 153件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 3件 締切済
- 通知発射: scan=1 nid / final=1 nid / result=0 nid
- predictions: 2 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 142R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=3.3 drift=+33.3% | 08:59:31 |
| S00 | 142R | win | 1 | 0.4111 | 4.4 | 1.81 | 300 | scan=- drift=- | 08:59:29 |
| S00 | 122R | win | 1 | 0.1034 | 4.7 | 0.49 | 300 | scan=- drift=- | 15:48:24 |
| S01_NAKAANA1 | 011R | win | 1 | 0.5123 | 4.7 | 2.41 | 200 | scan=- drift=- | 15:19:14 |
| S01_NAKAANA1 | 024R | win | 1 | 0.5735 | 4.7 | 2.70 | 200 | scan=- drift=- | 12:04:25 |
| S00 | 174R | win | 1 | 0.5123 | 6.1 | 3.13 | 300 | scan=7.5 drift=-18.7% | 11:32:23 |
| S02_TETSUBAN | 212R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=2.2 drift=+0.0% | 09:09:14 |
| S00 | 136R | win | 1 | 0.5891 | 4.8 | 2.83 | 300 | scan=- drift=- | 12:57:00 |
| S01_NAKAANA1 | 225R | win | 1 | 0.5735 | 4.3 | 2.47 | 200 | scan=- drift=- | 12:44:23 |
| S01_NAKAANA1 | 045R | win | 1 | 0.3177 | 4.6 | 1.46 | 200 | scan=- drift=- | 12:38:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 16 | +2.5% | -25.0% | +55.6% | 6 | 0 | 9 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 369.9s |
| **Latency** (scan→final max) | 530.9s |
| **Traffic** (notifications 24h) | 31 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 208 | 0.4768 | 0.3125 | +0.1643 | 🟡+34% | 0.2340 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 80 | 0.4343 | 0.2500 | 0.2131 | 🔴-0.14 | 0.62 |
| S01_NAKAANA1 | win | 89 | 0.4828 | 0.3258 | 0.2376 | 🔴-0.08 | 0.835 |
| S02_TETSUBAN | win | 39 | 0.5506 | 0.4103 | 0.2688 | 🔴-0.11 | 1.179 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 80 | 0.4120 | 0.3000 | 🔴+0.1120 |
| 0.50+ | 118 | 0.5472 | 0.3475 | 🔴+0.1997 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 208 | 0.818 |
| win | <5.0 | ✅learned | 378 | 0.737 |
| win | <10.0 | ✅learned | 160 | 0.449 |
| win | <20.0 | ✅learned | 48 | 0.252 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-11-23T09:00:02.345303+09:00_